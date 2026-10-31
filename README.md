# Ineltech IDiS Flash

Windows x64 desktop application for configuring and programming Ineltech IDiS devices based on Texas Instruments C2000 DSPs. It combines a Flutter interface with a native C++ flashing backend and distributes installers only; application source code is maintained in a separate repository.

## Slovenčina

### Čo aplikácia robí

Ineltech IDiS Flash slúži na prípravu a vykonanie flashovania podporovaných DSP zariadení cez sériový SCI bootloader. Grafické rozhranie spravuje viac flashovacích targetov a natívny backend komunikuje so zariadením, nahráva kernel a programuje aplikačný súbor.

- Načíta, vytvára a upravuje XML konfigurácie s viacerými targetmi.
- Pre každý target nastavuje COM port, baudrate, kernel a aplikačný TI `.out` súbor.
- Umožňuje flashovať všetky povolené targety alebo vybraný target a zobrazuje stav a priebeh operácie.
- Zobrazuje COM porty, verziu firmware a live bit; kontrolu možno zapnúť alebo vypnúť samostatne pre každý port.
- Poskytuje akcie Reset a Flash/Boot a ukladá logy a výsledky do používateľského AppData.
- Podporuje kernelové súbory pre TMS320F28334 a TMS320F28335.

### Inštalácia

1. Otvor [najnovší release](https://github.com/tfeeee/Ineltech-IDiS_Flash/releases/latest).
2. Stiahni `IDiS_Flash_Setup_<verzia>_x64.exe` a zodpovedajúci `.sha256` súbor.
3. Pred spustením over SHA-256 v PowerShelli:

   ```powershell
   $installer = '.\IDiS_Flash_Setup_<verzia>_x64.exe'
   $expected = (Get-Content "$installer.sha256").Split(' ')[0]
   $actual = (Get-FileHash $installer -Algorithm SHA256).Hash.ToLowerInvariant()
   if ($actual -ne $expected) { throw 'SHA-256 nesúhlasí' }
   ```

4. Spusti inštalátor. Windows môže vyžiadať potvrdenie UAC, pretože aplikácia sa inštaluje do `Program Files`.

### Aktualizácie a dáta

Aplikácia kontroluje GitHub Releases pri štarte a umožňuje kontrolu aj cez tlačidlo **Aktualizácie**. Pred inštaláciou zobrazí poznámky k vydaniu a vyžiada potvrdenie. Stiahnutý inštalátor sa overí podľa SHA-256 digestu z GitHub API a nespustí sa, ak kontrola zlyhá. Aktualizácia môže vyžiadať UAC.

Používateľské konfigurácie, nastavenia, logy a výsledky v AppData zostávajú pri aktualizácii zachované.

## English

### What the application does

Ineltech IDiS Flash configures and programs supported DSP devices through a serial SCI bootloader. Its Flutter desktop interface manages multiple flash targets while a native C++ backend communicates with the device, uploads the kernel, and programs the application image.

- Loads, creates, and edits XML configurations containing multiple targets.
- Configures a COM port, baud rate, kernel, and TI `.out` application file for each target.
- Flashes all enabled targets or an individual target and displays per-target status and progress.
- Shows detected COM ports, firmware version, and live bit; monitoring can be enabled or disabled for each port independently.
- Provides Reset and Flash/Boot actions and stores logs and results in the user's AppData directory.
- Includes kernel files for TMS320F28334 and TMS320F28335.

### Installation

1. Open the [latest release](https://github.com/tfeeee/Ineltech-IDiS_Flash/releases/latest).
2. Download `IDiS_Flash_Setup_<version>_x64.exe` and its matching `.sha256` file.
3. Verify the SHA-256 checksum in PowerShell before running the installer:

   ```powershell
   $installer = '.\IDiS_Flash_Setup_<version>_x64.exe'
   $expected = (Get-Content "$installer.sha256").Split(' ')[0]
   $actual = (Get-FileHash $installer -Algorithm SHA256).Hash.ToLowerInvariant()
   if ($actual -ne $expected) { throw 'SHA-256 mismatch' }
   ```

4. Run the installer. Windows may request UAC approval because the application installs under `Program Files`.

### Updates and user data

The application checks GitHub Releases at startup and also provides a manual **Updates** action. It displays the release notes and asks before installing. The downloaded installer is verified against the SHA-256 digest from the GitHub API and is not launched if verification fails. UAC approval may be required.

User configurations, settings, logs, and results stored in AppData are preserved during updates.