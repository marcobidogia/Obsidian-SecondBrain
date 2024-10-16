---
tags:
  - coding
  - cyber-security
---

## Security: Not an Add-On
Mentre l'umanità diventava man mano più connessa attraverso computer, telefoni ed internet gli attacchi informatici erano sempre più frequenti.
Le applicazioni target di questi attacchi erano di diversi tipi normalmente atti a rubare milioni di dati personali, carte di credito e dati sensibili.
Data questa crescita esponenziale i governi cominciarono ad aggiungere layer su layer di sicurezza.
Di base bisogna assumere l'atteggiamento di pensare che nulla a livello informatico è completamente sicuro, le vulnerabilità sono ad ogni angolo. Per rendere la vita degli attaccanti più difficile sarà necessario eseguire vari test per provare la sicurezza dei sistemi informatici che vengono prodotti.

## CIA Triad (Confidentiality, Integrity, and Availability)
I praticanti di Cybersecurity sono normalmente familiari con i principi della gestione della sicurezza e dei principali concetti. CIA Traid semplifica i principali obiettivi della Cybersecurity.
I principi su cui si basa sono:
- Confidentiality
- Integrity
- Availability
Per valutare i rischi e le vulnerabilità dell'organizzazione vengono valutati questi 3 principi insieme.

### Confidentiality

> [!info] Definizione
Preserving safeguards, access controls, and disclosures of sensitive data to ensure privacy (aka confidentiality) of personal and proprietary information from unintended parties.
Semplificato: Solo gli individui, processi e sistemi che devono accedere all'informazione la accederanno.
I dati devono mantenere questo principio in 3 fasi di processo:

#### 1. In storage
I dati presenti salvati in qualsiasi forma devono essere sicuri e confidenziali. Questo include che gli HDD, SSD, USB, SD e il cloud devono proteggerli e non renderli pubblici.

#### 2. In process
Quando i dati sono raccolti da un processo che li lavora devono essere a loro volta assicurati nella memoria volatile dove sono salvati. Potrebbero essere presenti dei malware o dei buffer overflow attacks che potrebbero continuamente analizzare la ram in cerca di questi.

#### 3. Traversing a network
I dati che passano attraverso protocollo HTTP devono almeno essere assicurati utilizzando la criptazione del protocollo stesso HTTPS.
La protezione di queste informazioni devono passare anche attraverso il principio #PoLP (principle of least privilege). Questo principio indica che l'accesso di dati o informazioni deve essere ristretto SOLO alle risorse assolutamente necessarie per performare il lavoro per il quale sono stati raccolti.

### Integrity

> [!info] Definizione
Guarding data/information, in transit or at rest, from unauthorized destruction or modification so that it remains in the state intended by the owner(s) upon receipt or submission. Ensuring the data/information is authentic and proven to be received from the true origin of the data/information (non-repudiation).
Semplificato: i dati devono essere quello che ci si aspetta che siano.
Nel computing l'integrità del dato/informazione è misurata dalla sicurezza che il dato sia autentico, accurato e sicuro da ogni accesso non autorizzato. Nell'information security invece se il meccanismo assicura l'integrità possiamo essere sicuri che il dato/informazione è inalterato dallo stato originale. Ovviamente come la Confidentiality deve essere assicurata at rest, in process e in transit.

#### Hashing
Uno dei metodi di base per garantire la sicurezza del dato è la crittografia hashing.
Attraverso la funzione di hashing verrà prodotta una valore hash univoco, simile ad un certificato di autenticità, poichè i dati produrranno sempre lo stesso hash se elaborati dalla stessa funzione.
l'Integrity del dato è oltretutto vitale per assicurarsi dell'autenticità del dato. Questa legata all'integrità del dato garantisce il concetto noto chiamato di non ripudio e garantisce di sapere l'identità dell'autore delle comunicazione e dei dati trasmessi.

### Availability
> [!info] Definizione
Ensuring that access to information, and the networked services that host the information, are accessible in a reliable and timely manner by users at all times.
Semplificazione: i dati devono essere disponibili quando lo dovrebbero essere.
Con Availability s'intende che i dati devono essere accessibili all'individuo/organizzazione al bisogno. Negare l'accesso alle informazioni è un concetto di Cybersecurity principale, per esempio gli attacchi DoS (Denial-of-Service) mirano a rendere inaccessibili le informazioni. Quando un'attacco DoS è in corso infatti verrà persa l'abilità di accedere a logs, software bugs, hardware failures utili per il funzionamento dell'app.

## Impacts of Cybersecurity Breaches
In questo modulo saranno specificate i principali impatti ad una breccia nel sistema informatico.

### Breaches, exfiltration, and data loss
Questi tre termini potrebbero sembrare simili ma in termini di sicurezza informatica vogliono dire:
- Data Breach: indica che dei dati sono stati esportati in modo non autorizzato e trasferiti all'interno del territorio nazionale.
- Data Exfiltration: indica che i dati sono stati esportati in modo non autorizzato e trasferiti all'esterno del territorio nazionale.
- Data Loss: indica che i dati non sono più reperibili in alcun modo, temporaneamente o permanentemente.

> [!Definition] Definizione
> Using terms from the CIA triad, data breaches and exfiltration are violations of confidentiality, while data loss is a violation of availability.
I data breach non hanno un peso tanto per l'azienda ma più per i clienti di questa. Infatti i dati  potrebbero essere usati per frodi, furti d'identità e molto altro.
Per l'organizzazione, aver sofferto di un data breach è un problema di reputazione.

### Prevention and response
Se i data breaches sono un male perchè non prevenirle? una domanda semplice che però ha una risposta molto più complessa. Purtroppo, anche se tutte le aziende applicassero le giuste precauzioni, purtroppo, ci sarebbe comunque la possibilità che venga trovata una nuova vulnerabilità ed utilizzata per entrare nei sistemi informatici. I professionisti della sicurezza devono sviluppare un approccio di sicurezza per prevenire gli incidenti al meglio possibile, imparando dagli incidenti che sono successi in passato.

## Common Cybersecurity Roles
La Cybersecurity è un industria in rapida espansione e contiene varie path di carriere. Qui di seguito ne saranno esposte alcune.

### Discipline 1: Incident Response (IR)
Incident Response, o IR, indica le attività di risposta dal momento della sospettata breccia fino al post-incident.
I "risponditori" tipicamente lavorando assieme al team e conoscono tutti gli aspetti maggiori della cybersecurity.
In accordo con il NIST ecco i principali step per assicurare gli incident:
- Preparazione
- Rilevamento e analisi
- Contenimento
- Eradicamento e recupero
- Post-incident activities

#### Job Titles
Normalmente i titoli di lavoro sono:
- Cyber Incident Response Analyst
- Incident Response Consultant
- Cyber Detection Analyst
- Insider Threat Response Analyst

#### Responsibilities
Il ruolo dell'IR è normalmente responsabile di trovare e valutare le minacce e gli incidenti informatici.

#### Required Skills
- An understanding of various security methodologies, processes, and technical security solutions (i.e. firewalls, proxies, and intrusion detection systems).
- Strong knowledge of various operating systems.
- A background in using different forensic analysis tools in incident response investigations is also helpful.

#### Educational Background
A Bachelor’s degree in a relevant field, such as Computer Science, Cybersecurity or Information Systems, or equivalent experience.
Equivalent experience can be gained from:
- Related work in cyber investigations.
- Training courses and certifications in incident response/digital forensics.
- Experience in the military, law enforcement, or the intelligence community.

#### Commonly Held Certifications
- CISSP (Certified Information Security Systems Professional)
- GCIH (GIAC Certified Incident Handler)
- GCFE (GIAC Certified Forensic Examiner)
- GCFA (GIAC Forensic Analyst)

### Discipline 2: Governance, Risk, and Compliance (GRC)
Individui che sviluppano e pianificano policy, procedure e piani per ridurre il rischio e monitorare la compliance con i regolamenti. Normalmente i usano i frameworks: NIST Cybersecurity Framework, ISO 27001, COBIT, FFIEC per assicurare la sicurezza e la gesione del rischio.

#### Job Titles
Job descriptions for this sort of role might include the following job titles:
- Cyber GRC Analyst
- Cyber GRC Consultant
- Cyber GRC Advisor
- Information Security Risk Analyst
- Information Security Risk and Compliance Analyst
Remember, this list is not all-inclusive!

#### Responsibilities
Cybersecurity GRC professionals work cross-functionally with other information security teams to identify and monitor risks to the business. They ensure that legal and regulatory requirements regarding cybersecurity and data privacy are understood and managed. GRC Analysts will conduct risk assessments that assess security controls across different domains and formulate appropriate risk scoring so potential business impacts and likelihoods are identified.

#### Required Skills
- Knowledge of regulatory and nonregulatory frameworks such as NIST, ISO, COBIT, DFS, FFIEC, to name a few.
- An understanding of various security methodologies, processes, and technical security solutions helps (i.e. firewalls, proxies, and intrusion detection systems), although deep technical expertise is not needed.
- Effective project and time management, as well as sharp analytical and communication skills, are essential.

#### Educational Background
A Bachelor’s degree in a relevant field, such as Business, Information Technology, Information Security, Computer Science, or Risk Management, or equivalent experience.
Equivalent experience can be gained from:
- Prior related work in risk management.
- Training courses and certifications in risk and project management.

#### Commonly Held Certifications:
- CISSP (Certified Information Security Systems Professional)
- CISM (Certified Information Security Manager)
- CISA (Certified Information Security Analyst)
- PMP (Project Management Professional)

### Discipline 3: Threat Intelligence
la Threat intelligence è un gruppo di professionisti atto a miticare potenziali vulnerabilità del software.

#### Job Titles
Job descriptions for this sort of role might include the following job titles:
- Cyber Threat Intelligence Analyst
- Security Researcher
- Threat Hunter
- Cybercrime Analyst
- Cyber Threat Investigator
Remember, this list is not all-inclusive!

#### Responsibilities
Cyber Threat Analysts can be responsible for providing strategic, tactical, and operational analysis before or during ongoing incidents. They will collect and analyze threat information from various sources and then convert that into finished reports and assessments. They work with other internal information security teams, third-party vendors, and industry partners to gather and share information that assists with incident response.

#### Required Skills
- Keen analytical skills and an ability to synthesize complex information from a variety of disparate sources.
- Knowledge of advanced persistent threats and key threat intelligence models such as MITRE is also highly recommended and sought after by hiring managers.
- Able to collaborate with external parties, including peer analysts and threat intelligence vendors.

#### Educational Background
A Bachelor’s degree in a relevant field, such as Information Security, Computer Science, Engineering, Threat Intelligence, or equivalent experience.
Equivalent experience can be gained from:
- Prior related work in government or military intelligence.
- Training and certifications in cyber threat intelligence.

#### Commonly Held Certifications:
- CISSP (Certified Information Security Systems Professional)
- GREM (GIAC Certified Reverse Engineering Malware)
- GCFE (GIAC Certified Forensic Examiner)
- CISA (Certified Information Security Analyst)

### Discipline 4: Security Operations
Questi specialisti offrono design, implementazione e manutenzione di controllori di sicurezza informatica. Lo scopo principale del personale addetto alle operazioni di sicurezza è salvaguardare le risorse, tra cui informazioni, sistemi, dispositivi e strutture. La gestione delle patch e delle vulnerabilità, nonché la gestione della configurazione, sono considerate fondamentali per le operazioni di sicurezza.

#### Job Titles
Job descriptions for this sort of role might include the following job titles:
- Security Operations Analyst
- Information Security Engineer
- Security Operations Center (SOC) Analyst
- Cloud Security Engineer
Remember, this list is not all-inclusive!

#### Responsibilities
Security Operations Analysts are typically responsible for security monitoring and incident management. They are also involved in the design, development, and implementation of software to optimize security operations. They perform reviews of all systems and applications, monitor security logs, and report any security concerns to senior members of the security operations team. Security Operations Analysts may also need to work cross-functionally with other internal cyber teams on vulnerability management and system architecture and configuration-related issues.

#### Required Skills
- Well-versed in the technical infrastructure of an organization.
- Have a solid understanding of security concepts applied to various operating systems, applications, networking, cloud, and mobile devices.
- Knowledge of SIEM, familiarity with attack frameworks and mitigation are also valuable skills to have for these types of roles.
- Depending on the specific role within security operations, it may be necessary to have skills in one of the following domains: Network Operations and Architecture, Operating Systems, Identity and Access Management, Programming, Cloud Computing, Databases, or Cryptography.

#### Educational Background
A Bachelor’s degree in a relevant field, such as in Information Security, Computer Science, Engineering, or equivalent experience.
Equivalent experience can also be gained from:
- Related work in a security operations center (SOC), military, or intelligence cyber operations.
- Training courses focused on cyber defense.

#### Commonly Held Certifications
- CEH (Certified Ethical Hacker)
- CompTIA Security+
- GSEC (GSEC)
- CISSP (Certified Information Security Systems Professional)
- CISM (Certified Information Security Manager)

### Discipline 5: Offensive Security
Spesso definiti tester della sicurezza informatica, questi sono gli individui che hackerano i sistemi per individuare problemi. Cercano lacune e vulnerabilità nella sicurezza prima che lo faccia un utente malintenzionato. I team offensivi di sicurezza informatica testano attivamente le difese della rete e forniscono informazioni preziose attraverso risultati tecnici e rapporti di riparazione.

#### Job Titles
Job descriptions for this sort of role might include the following job titles:
- Pen Tester
- Threat Hunter
- Red Teamer
- Cybersecurity Tester
- Exploit Developer
- Ethical Hacker (sometimes known as a “white hat” hacker)
- Vulnerability Researcher
Remember, this list is not all-inclusive!

#### Responsibilities
Offensive security professionals actually attempt to exploit systems. They try to defeat security controls and break into a targeted system or application to demonstrate the flaw. They will document and formally report testing initiatives, along with remediation recommendations. Pen Testers/Red Teamers must stay up to date on the latest malware and design new testing methods to identify vulnerabilities.

#### Required Skills
- Possess deep technical knowledge of cybersecurity concepts.
- Have coding and programming skills as pen testing often requires specialized tools and techniques.
- Familiarity and knowledge of offensive security tools and frameworks such as Metasploit, BurpSuite, CoreImpact is often required.
- The ability to articulate complex technical findings to different audiences, often in the form of written reports, is also a key skill.

#### Educational Background
A Bachelor’s degree in a relevant field, such as Computer Science, Information Security, Information Technology, Cybersecurity, or equivalent experience.
Equivalent experience can also be gained from:
- Prior related work.
- Training courses and certifications in cybersecurity.
- Experience in the military, law enforcement, or intelligence community.

#### Commonly Held Certifications:
- CEH (Certified Ethical Hacker)
- GPEN (GIAC Penetration Tester)
- GXPN (GIAC Exploit Researcher and Advanced Penetration Tester)
- GWAPT (GIAC Web Application Penetration Tester)
- OSCP (Offensive Security Certified Professional)
### Discipline 6: Data Privacy & Protection

#### Job Titles
Job descriptions for this sort of role might include the following job titles:
- Data Privacy Analyst
- Data Privacy Consultant
- Data Privacy Officer
- Privacy and Compliance Analyst
Remember, this list is not all-inclusive!

#### Responsibilities
Data privacy analysts will support the development and implementation of privacy plans, policies and procedures. They will research and stay abreast of new developments in the legal and privacy realm, work with other internal teams, and identify risks to personal and confidential data.

#### Required Skills
- Strong research, writing, analytical, and critical thinking skills as well as project management capabilities.
- Knowledge of basic privacy laws, regulations, and control frameworks (CCPA, GDPR) is often desired.

#### Educational Background:
A Bachelor’s degree in a relevant field, such as Law, Information Systems, Information Security, Cybersecurity, or equivalent experience.
Equivalent experience can also be gained from:
- Prior related work
- Training courses and certifications in cybersecurity
- Experience in the military, law enforcement, or intelligence community.

#### Commonly Held Certifications:
- CIPP/US (Certified Information Privacy Professional/United States)
- CIPP/E (Certified Information Privacy Professional/Europe)
- CIPM (Certified Information Privacy Manager)
- CIPT (Certified Information Privacy Technologists)