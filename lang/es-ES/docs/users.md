# Guía para Jugadores con Mods

Si tú juegas "Vanilla/Vainilla" **solo** con un lanzador confianza como el lanzador oficial o Prism, y nunca has tocado mods: estás 100% seguro. Mantente alejado de los mods por ahora.

Si estás un jugador de Minecraft con mods, necesitas verificar si has estado infectado por el malware fractureiser para asegurar tu máquina/computadora y datos personales no están en riesgo. Puedes hacerlo con las instrucciones abajo.

### ¿Todavía está pasando?
**No. Bueno, un poco.**  
A partir de ahora, con nuestro conocimiento actual, creemos que el virus `fractureiser` se ha limpiado por completo de los mod(pack)s públicos actuales.

Nuestra recomendación actual es que los jugadores que hayan ejecutado el verificador de etapa 2 en esta página estén seguros para continuar jugando, sin embargo, ya que las cargas de mods se han vuelto a poner en línea tanto en CurseForge y Modrinth, ahora existe la posibilidad de que los autores de malware de imitación creen nuevos virus.

Estamos en contacto con todas las partes relevantes para establecer protocolos para que esto no vuelva a suceder en el futuro.

Si desea jugar, siga los pasos de diagnóstico de esta página, así como las siguientes secciones sobre qué hacer si está infectado o no.

### Estructura de la Página
* [¿Qué fue lo que sucedió?](#qué-fue-lo-que-sucedió)
* [Am I Infected?](#am-i-infected)
* [I'm Infected, Now What?](#im-infected-now-what)
* [I'm Not Infected, Now What?](#im-not-infected-now-what)
* [Frequently Asked Questions](#frequently-asked-questions)
* [Technical FAQ](#technical-faq)

Si tienes preguntas sobre fractureiser, por favor lee esta página completa, incluyendo las preguntas frecuentes al final, ya que la mayoría de las preguntas que hemos estado recibiendo están respondidas aquí.

## ¿Qué fue lo que sucedió?

El creador del malware cargó inicialmente varios mods y complementos maliciosos de aspecto inocente al sitio web de alojamiento de mods CurseForge y al centro de complementos dev.bukkit.org (no al código de Bukkit en sí). Un desarrollador de paquetes de mods de alto perfil descargó uno de estos mods para probar que infectaba archivos en su computadora sin su conocimiento - esto incluía una copia de un proyecto de trabajo que luego se cargaría en CurseForge como un archivo aparentemente legítimo, con el virus incluido.

Este proceso luego se repitió para algunos otros casos de usuarios en CurseForge y dev.bukkit.org, infectando copias de varios plugins y mods populares. *Hay reportes de plugin malicioso y mod jars desde mediados de abril.*

Además de esto, el autor del malware intentó acceder por fuerza bruta a cuentas de creadores de contenido de alto tráfico en CurseForge. Actualmente no estamos seguros de si la infracción se debió a un intento de fuerza bruta o a una infección troyana en los propietarios de las cuentas.

Este malware se compone de múltiples "etapas", cada etapa es responsable de descargar y ejecutar la siguiente. En total, hay tres etapas conocidas (etapas 1, 2 y 3), con archivos de mods infectados que sirven como "Etapa 0" para iniciar todo el proceso.

La etapa 3 es la "mente maestra" del malware y tenemos pruebas de que intenta hacer todo lo siguiente:

* Se propaga a *todos* los archivos `jar` en el sistema de archivos, posiblemente infectando mods que
  no se descargaron de CurseForge o BukkitDev, u otros programas Java
* Robar cookies e información de inicio de sesión de muchos navegadores web
* Reemplaza las direcciones de criptomonedas en el portapapeles con alternativas que presumiblemente sean propiedad de
el atacante
* Robar credenciales de Discord
* Robar credenciales de Microsoft y Minecraft

(See [technical details](tech.md) for more info)

Debido a su comportamiento, estamos **muy seguros** de que se trata de un **ataque dirigido contra el ecosistema de Minecraft modificado**. Esto es bastante malo.

**Until further notice, exercise extreme caution with Minecraft mod downloads, regardless
of origin.** While the control server for this malware is currently offline, **any
download from Curseforge or the Bukkit plugin repository in the last 2-3 weeks should be
treated as potentially malicious**. Some malware scanners have started adding signatures
to their databases, but until this rolls out to all of them, please exercise caution.

*At this point we cannot be confident claiming any hosting service is unaffected*. Please
exercise caution regardless of what site you use. Even Maven repositories may be infected,
and this malware goes back months.

Currently, new infections are impossible as the attacker's server has been shut down,
existing infections may still be active.

<!--### Get to the point, how do I fix this?

![Flowchart](media/flowchart.png)-->

### Wait, what the f*** is a "stage"?

![Stage Diagram](media/stages.png)

## Am I Infected?

The malware has multiple stages, so asking whether you are infected is actually two questions

### Do any of my mod files have Stage 0?
A variety of scanners exist that take a mod file and detect whether it is infected by Stage 0 of
the malware.

* Overwolf's [scanner](https://github.com/overwolf/jar-infection-scanner/releases)
  * This is the recommended option for checking your entire game - just point it at the CurseForge 
installation folder or wherever else  you have your instances saved
  * This is a standalone program and does not require the Overwolf app installed
* douira's [website-based online scanner](https://douira.github.io/fractureiser-web-detector/)
* cortex's [nekodetector](https://github.com/MCRcortex/nekodetector/releases) 
  * Click on "Assets" to show the runnable file - requires Java to be installed

In isolation, stage 0 infection is not dangerous if the files are deleted and never ran.

### Are Stage 2 files present on my system?

Stage 2 files being on your system means that the stages 0 and 1 of the malware ran successfully.
If they are present at all, you are likely *fully infected* and should continue reading the
instructions in the document.

Many virus scanners are starting to detect stage 2 files. If you get a warning that such
files were found and removed, proceed to the "I'm Infected, Now What?" section.

Otherwise, you can check manually by doing the following, based on your platform:

#### Windows Instructions

* Open your Start menu with the Windows Key, and type `%localappdata%` - it should appear as such:
![Search results for the above query](media/localappdata.png)

* Inside the Local appdata folder, you must ensure that your Explorer is set to view both 
`Hidden Items`, and `Protected Operating System Files`.
  * This can be done from View > Options
  * If you are unsure how to do this, a video explanation 
[can be found here](https://youtu.be/KLTlTlnXeKs).
  * Windows 11 users can find the same options under the "View" button at the top ribbon, as 
  well as  the  "..." button on the rightmost side of it

* Locate a folder named `Microsoft Edge`. The SPACE between "Microsoft" and "Edge" is
  important - as `MicrosoftEdge` is a legitimate folder that is used by Edge.  The virus
  simply named it like that to disguise itself.  
  * The legitimate folder might also be called `Microsoft\Edge` (an `Edge` folder inside a 
`Microsoft` folder).
  * The legitimate folder doesn't *have* to exist - if you don't have any Edge related folders,
  you're safe.
  * Both legitimate folders can exist at the same time, this is okay too.
* If `Microsoft Edge` is present, you were infected. If this is the case, permanently delete the 
folder and everything inside it.
  * If the folder can not be deleted, you must stop any Java programs currently running via your 
Task Manager.

#### MacOS Information

The malware does not seem to affect MacOS, so you should be fine.  
*Check back here every now and then just in case.*

#### Instrucciones Linux

Firstly, ensure whichever method you are using to list files has the ability to view hidden files.
Most GUI file managers have the shortcut Ctrl+H to toggle hidden files. If doing this on a terminal, 
use `ls -A` in the respective directories, or `ls -lha` for a more detailed listing.

If any of the following files exist, you were infected. If this is the case, delete all of them:
* `~/.config/systemd/user/systemd-utility.service`
* `/etc/systemd/system/systemd-utility.service`
* `~/.config/.data/lib.jar`

Upon doing so, if applicable, check your `journalctl` for any changes you may not recognize. You
can do this with the commands `journalctl -exb` (for system logs) and `journalctl -exb --user` 
(for user logs). Run the following commands to refresh your systemd services:
```sh
sudo systemctl daemon-reload # Enter your user password
systemctl --user daemon-reload 
```

#### Scripts

*If you don't know how to run a PowerShell or Bash script, these are not for you.*  
Automated PowerShell or Bash scripts are also available [on the PrismLauncher
website](https://prismlauncher.org/news/cf-compromised-alert/#automated-script) to check
for Stage 2 for you, if you have the technical knowhow to run them. Overwolf (Curseforge's
parent company) has also released a C# Stage 2 detection tool:
https://github.com/overwolf/detection-tool

## I'm Infected, Now What?

**IMPORTANT**: We do not currently know the full extent of everything this can do, nor what its
intent is, so extreme caution should be exercised until a complete way to remove any symptoms is
found. Everything stated here is only *what we know* - please keep an eye on communication from the
team on updates if anything critical is found.

If you find stage 2 files from fractureiser on your system, it's very likely that the stage 3 code
has ran and infected your machine.  
Your best option now is to assume everything on that system is *entirely compromised*. You should:

* Back up anything you do not want to lose on an a flash drive or external disk (you should be
doing this regularly anyway!)
* Using a separate device, change the passwords to all services you were logged into on
  the old machine (Discord, email, etc.). Preferably using a password manager like
  [BitWarden](https://bitwarden.com).
* If you were not yet using Two-Factor Authentication (Authenticator app or SMS) for every service
that supports it, please start doing so immediately
* If you are able to, contact a professional service in your area to run a proper
  diagnostic on your machine for anything suspicious, or as a safe default simply wipe and
  reinstall the system.
* Read the below section on what to do if you're not infected, as the steps there apply to you too.

## I'm Not Infected, Now What?

If you have played mods in the last few months, the absolute safest thing you can do at the moment 
is to **not launch Minecraft at all**. Yes, even Vanilla.  

With that said - if nothing was found in the first place, chances are there's nothing going on.
If you still want to play the game:
* With the current knowledge we have, this is not risky, but we do not guarantee this is
accurate - you are *willingly putting yourself at risk*.
* After each session, check for the stage 2 infection files in the previous step to ensure nothing
has happened since
* Do not, under **any circumstances**, download or update any mods, modpacks, or plugins you
may use, or even run any you downloaded and never ran before - stick to instances you have
already used, and those **ONLY**.

## Frequently Asked Questions

### Is CurseForge hacked?
CurseForge itself is not compromised, only individual users. This is not a CurseForge problem, they
just happened to the be place this happened in. CurseForge have also [posted an article](https://support.curseforge.com/en/support/solutions/articles/9000228509-june-2023-infected-mods-detection-tool/) describing the situation from their end and
are working on deploying countermeasures.

### Is Modrinth okay?
Modrinth has ran a full scan of the last 10 months of uploads and no infected projects were found. 
We still recommend exercising extreme caution when downloading anything mod related at the moment. 
The fact no mods were infected there was entirely luck.

### Is Modrinth safer?
This isn't a website-level issue, Modrinth is just as safe as CurseForge is.

### How did CurseForge let this slip through?
The code the stage 0 infection ran wasn't necessarily suspicious to an automated system, and could
very well have been something another mod would've used. In fact, early heuristics for determining
stage 0 infection had significant amounts of false flags on popular mods such as Quark.

Realistically, this type of prevention on a platform scale is non-feasible due to the infinite
different ways you can lay out code to hide your intent.

### Which Antiviruses catch this?
New ones are being added as we speak, it's best to do the manual verification above instead of
relying on AV for now.

### Is Multiplayer safe?
Yes, you can not be infected via a multiplayer server if you don't download mods for it elsewhere.

### Is Bedrock safe?
Yes, this affects only Java.

### Are alternative game clients such as Lunar or Badlion safe?
See the below point.

### Is Optifine safe? / Is Sodium safe? / Is Iris safe? / Is Create safe? / Is Essential safe? / Is (insert mod) safe?

**We can not currently fully confirm the safety of any given mod.**

One of the functions of stage3 of the virus is infecting as many .jars as it can find on your 
computer. It can infect **all `.jar`s**, including Minecraft itself (vanilla/modded), Minecraft 
mods, Spigot plugins, and unrelated Java applications. So if your computer has the stage3 portion 
of the virus, it doesn't matter whether a mod you download is "safe" - it will *become* infected. 
Detect and remove the later stages of fractureiser *first*.

At the moment, all *known* infected mods have been removed from CurseForge. CurseForge [posted a 
list of known infected mods](https://support.curseforge.com/en/support/solutions/articles/9000228509-june-2023-infected-mods-detection-tool/) (bottom
of the page) and has removed them from the website. Modrinth has scanned back 10 months and has not found any infected mods. 

This does *not guarantee no sneaky ones slipped through*. To check whether a given jar contains 
stage0 of fractureiser, check the [Am I Infected?](#am-i-infected) section and overall exercise
extreme caution downloading anything mod related for now.

### How widespread was the infection?

CurseForge is reporting infected files were downloaded roughly 6,000 times for the entire 
infection period. Quote from CF's Discord announcement: 
> Just to give perspective, this accounts to about 0.015% of CurseForge’s daily downloads 
> for Minecraft.

### Did someone want to spoil the 1.20 release event?

It appears to be a coincidence - this malware campaign was active for quite a while before being 
widely uncovered the morning-of the 1.20 release.

## Technical FAQ

### Can fractureiser escape VMs (Virtual Machines)?

**No.**

stage3 *does* contain code for *attempting* a *manual* escape from the 
["Windows Sandbox"](https://learn.microsoft.com/en-us/windows/security/application-security/application-isolation/windows-sandbox/windows-sandbox-overview).
It does not happen automatically. If the virus is ran from the Windows Sandbox, it will try to
mess with the clipboard to trick you into pasting a shortcut to the malware.

Note that this sort of "clipboard escape" is nothing new and it is very easy to defeat by simply
not sharing the clipboard between the host and guest OS. Use a more heavyweight virtual-machine
than the "Windows Sandbox", and disable features like VirtualBox's "Guest Addons" or Hyper-V's
"integration services".

(*Real* virtual-machine escape exploits are worth millions of dollars and would not be burned on
some Minecraft kids, and we have reason to believe the author of this malware is not a very good
programmer in the first place.)

### Does this spread over the network?

As far as we know, fractureiser does not contain network spread functionality, but it is not fully
out of the question.  
A security researcher we are working with got an alert, but it ended up being about completely 
unrelated malware that happened to use a similar filename. This was just a false alarm.

### What are CurseForge and Modrinth doing about it?

CurseForge has developed an open-source [stage2/3 detection tool](https://github.com/overwolf/detection-tool) 
and [stage0 detection tool](https://github.com/overwolf/jar-infection-scanner), have scanned *all* 
uploaded mods/plugins for stage0 infections, and have deleted all *known* infection cases.

Modrinth has also scanned uploaded mods/plugins for stage0 infections going back 10 months and did 
not find any.

Both platforms are considering introducing some sort of automated "virus scan" process to the mod 
submission pipeline. It's hard, since Java malware like this is typically bespoke.

### What IP addresses and URLs should I block in my firewall/routing table?

fractureiser-related code has been observed to connect to these URLs and addresses over a wide 
variety of port numbers.

* The hardcoded address in stage0-infected mods, and the first observed command&control 
server: `85.217.144.130`
* The second observed command&control server: `107.189.3.101`
* The fallback URL that stage1 tries to use, and the stage2 command&control hostname: 
`files-8ie.pages.dev`

There's also evidence of it trying to connect to the hostname `v2202209151437200088` 
over port 25575 - unknown reasons; probably from an older version of the malware.

Here are some additional addresses to firewall related to skyrage stuff (again, *very* unlikely 
skyrage was downloaded to anyone's PC through this vector, but nothing good comes from these 
addresses anyway):

* `95.214.27.172`
* `connect.skyrage.de`
* `t23e7v6uz8idz87ehugwq.skyrage.de`
* `qw3e1ee12e9hzheu9h1912hew1sh12uw9.skyrage.de`
* *Probably just block all of `skyrage.de` honestly*

Should go without saying that you should not visit these.

### Can we make it against CurseForge/Modrinth rules for your mod to download other files?

It's already against CurseForge rules to upload malware. There are also many legitimate use cases 
for a mod to download files that this would also stifle.

### Would it be possible to include some sort of "antivirus" or "sandbox" in the modloader itself?

"Antivirus": Probably not, for the same reasons that regular antiviruses didn't detect it. 
Antiviruses can only detect known malware, not unknown malware.

Sandboxing: Including some sort of "does this class contain 'safe' code?" check before loading a 
class is a great way to spur on a cat-and-mouse game between malware developers and modloader 
developers.

It's really hard to ban Java code from using a specific class (say, `URLClassLoader`) because you 
can also refer to it with `Class.forName` (which has a ton of legitimate use-cases), and if you 
ban or deny-list classes from *that*, you can typically find something *else* on the classpath 
willing to call `Class.forName` for you, and trying to get rid of these gadgets is an endless 
game of whack-a-mole.

Sandboxing Java is pretty much impossible - see articles like 
["Twenty Years of Escaping the Java Sandbox"](https://www.exploit-db.com/papers/45517).

Java mods are simply bundles of arbitrary code: treat them like an `.exe`, they can do anything. 

### Why aren't mods cryptographically signed to prevent malware from tampering with them?

Part of the problem is that signatures alone do not prevent malware - a cryptographically-signed 
virus is still a virus - and if self-signing was permitted, it doesn't prevent tampering either - 
it's possible for a virus to simply strip digital signatures off a jar ("delete META-INF") and 
re-sign it with its own key. (This isn't a hypothetical, either: fractureiser does contain code to 
remove digital signatures from the jars it infects.)

Signed mods with online signature verification *does* seem like a somewhat promising way forward, 
though it's not without tradeoffs. There will be [a meeting](2023-06-08-meeting.md) with
many different reps from the modding ecosystem to discuss how to move forward.

### Would it be possible to forbid mods from downloading executable code?

It's not possible. You can't know whether a file contains executable code before you download it, 
and after a file is downloaded, you can't control what is done with it.

* What if my mod downloads a single Java class file?
* What about a Java class file but spelled backwards, so it doesn't look like a class file at first?
* What about a Java class file but encrypted?
* What about Java *source* code that is compiled on your computer?
* What about a Python script?
* What about a file containing English prose where it just so *happens* that sentences with an 
even number of words correspond to a 0, and sentences with an odd number of words correspond to 
a 1? - even though it's a prose document I can technically reassemble it into 
an `.exe`, if I so choose.

### Is this related to that Spigot plugin malware going around?

Possibly! There's some ties to the existing malware `skyrage` - the malware author uploaded a 
skyrage-relevant `.jar` to their backup command&control server, in a fruitless attempt to 
extend the attack, shortly before CloudFlare took it down anyway.

**We have not received any reports of anyone becoming infected by Skyrage through this vector.** 
The author updated their CloudFlare URL to point to Skyrage a significant length of time *after* 
the hardcoded IP address in stage0-infected mods was already taken down. It's mostly a funny 
curiosity that the attacker tried to serve this jar at all.

skyrage is an existing, well-studied piece of malware and you can find some more info about 
it [here](https://ljskatt.no/analysis/updater_class/).
