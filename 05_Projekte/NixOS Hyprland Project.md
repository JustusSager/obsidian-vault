Bei NixOS werden alle Änderungen am Basis OS über verschiedene Konfigurationsdateien gemacht. Das schließt z.B. auch das installieren von Software ein.

Die Basisdatei liegt unter:
`/etc/nixos/configuration.nix`

NixOS Configuration neu laden:
``` bash
// neu laden und direkt starten
nixos-rebuild switch --use-remote-sudo

// neu laden und als test starten
// reboot setzt configuration zurück
nixos-rebuild test --use-remote-sudo

// beim nächsten reboot neu laden
nixos-rebuild boot --use-remote-sudo
```

# Desktop Umgebung
Zu einer Desktop-Umgebung gehören viele Komponenten die man bei anderen Betriebssystemen gar nicht beachtet und als selbstverständlich wahrnimmt. Hier einmal aufgelistet welche Komponenten noch händisch mitinstalliert werden müssen und welche Alternativen es so gibt.

## Terminal
Als erstes Terminal (und standardmäßig auch vorkonfiguriert) habe ich `kitty` ausprobiert. Jedoch fanden meine ersten Versuche in einer VM statt (was ich mit NixOS und Hyprland nicht empfehlen kann) und dort gab es mit `kitty` Probleme mit den 3D-Graphiken die dabei verlangt werden. Daher habe ich mich als Grundlage erstmal für `foot` entschieden, da es bereits in der VM funktionierte und bisher alles erfüllt was ich von einer Konsole gerne hätte.
## Terminal Text Editor
Hier habe ich folgende installiert:
- nano (ist bei NixOS standardmäßig vorkonfiguriert)
- vim
## File Manager
Hier habe ich folgende ausprobiert:
- `dolphin` (ist bei NixOS standardmäßig vorkonfiguriert)
#TODO hier vervollständigen
## App-Launcher

## Task Bar
Als Task/Status-Bar verwende ich `waybar`.
## Copy-Paste

## Web Browser

## Logout / Shutdown GUI
#TODO noch konfigurieren
- `wlogout`
- 

## Notification Daemon
Manche Apps wie Discord stürzen ab, wenn kein (mit dieser App) kompatibler Notification Daemon installiert und aktiviert ist.

Hierfür verwende ich `mako`, jedoch muss sich noch zeigen, ob es den Zweck erfüllt.


# Softwareentwicklung mit NixOS und Hyprland ^9bf76f
Es gibt viele Dinge, die unter Hyprland gut funktionieren. Die Entwicklung von Software, welche auf den X11 Server angewiesen ist leider nicht. 
Bei diesem Projekt durfte ich inzwischen lernen, dass die Entwicklung einer Graphischen Benutzeroberfläche stark davon abhängig ist, welche Art von Window Manager man hat. Leider bin ich ausgerechnet auf Software und Libraries angewiesen, die unter dem Window Manager von Hyprland gar nicht oder nur Eingeschränkt funktionieren. 
Um dennoch weiterhin (zumindest als Basisbetriebssystem und Window Manager) NixOS und Hyprland verwenden zu können, wird der Teil meiner Softwareentwicklung, welcher unter Hyprland nicht funktioniert (C++ Programmierung mit der SFML Library und QGIS Python-Plugin Entwicklung) in eine [[#^69831e|Virtuelle Maschine]] unter Ubuntu ausgelagert.
Immer das positive sehen, dafür habe ich jetzt (gezwungenermaßen) eine Spielwiese in der ich alles ausprobieren kann, ohne dass es man Hauptsystem beeinflusst. 
Das könnte langfristig jedoch doch dazu führen, dass ich doch auf einen anderen Window Manager wechsle, falls nur dass das Problem ist. Mit NixOS kann ich mich dennoch gut anfreunden.

# Software

## VirtualBox ^69831e
VirtualBox lässt sich über die `/etc/nixos/configuration.nix` einfach installieren. Man muss einfach innerhalb der äußersten Klammern folgendes eingeben:
```
virtualisation.virtualbox.host.enable = true;
virtualisation.virtualbox.host.enableExtensionPack = true;
users.extraGroups.vboxusers.members = [ "<nutzername>" ]
```
Nach einem reload war VirtualBox installiert. 
Bei dem Versuch Ubuntu als VM zu installieren sind jedoch direkt die ersten Probleme aufgetaucht. Scheinbar darf man `virtualbox` nicht unter `environment.systemPackages` auflisten. Das hat NixOS scheinbar verwirrt in Bezug auf die Berechtigungen, die VirtualBox hat, wodurch sich keine VM starten ließ. Eine Google Recherche später war das Problem behoben und die VM schien zu funktionieren.

Zumindest solange man nicht den Vollbildmodus nutzen wollte. Sobald man in den Vollbildmodus gewechselt ist wurde nur noch Schwarzbild angezeigt. Nach einer kurzen Recherche ließ sich jedoch herausfinden, dass sich dieser Bug beheben lässt, indem man die Menüleiste, die im Vollbildmodus um unteren Rand als PopUp-Menü eingeblendet wird, deaktiviert. Das lässt sich in den Einstellungen der VM schnell machen und hat auf anhieb funktioniert. Nur die Shortcuts muss man jetzt auswendig können um aus diesem Vollbildmodus auch wieder rauszukommen.

Jetzt scheint es, als könnte ich loslegen die Ubuntu VM aktiv zur [[#^9bf76f|Softwareentwicklung]] zu nutzen.
# Hyprland nach der Anmeldung mit tty1 ausführen
https://www.youtube.com/watch?v=fmFjV3_iIn0&t=465s (9:00 Min)
``` bash
echo '[[ "$(tty)" == "/dev/tty1" ]] && exec Hyprland' >~.bash_profile
```

# Flakes 
#TODO Was sind Flakes und warum musste ich es aktivieren?
https://drakerossman.com/blog/how-to-convert-default-nixos-to-nixos-with-flakes

## Flakes aktivieren:
Eine neue Datei anlegen:
`/etc/nixos/flake.nix`
mit folgendem Inhalt:
``` bash
{
  description = "flake for yourHostNameGoesHere";

  inputs = {
    nixpkgs = {
      url = "github:NixOS/nixpkgs/nixos-unstable";
    };
  };

  outputs = { self, nixpkgs }: {
    nixosConfigurations = {
      yourHostNameGoesHere = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
        ];
      };
    };
  };
}
```
`yourHostNameGoesHere` ersetzen durch den entsprechenden Hostname, zu finden unter `/etc/nixos/configuration.nix`

Oben in der `/etc/nixos/configuration.nix` folgendes einfügen (innerhalb der äußersten geschweiften Klammern)
``` bash
nix = {
  package = pkgs.nixFlakes;
  extraOptions = ''
    experimental-features = nix-command flakes
  '';
};
```

Mit folgendem neu laden (mit sudo, während man in `/etc/nixos` ist)
`nixos-rebuild --flake .#yourHostNameGoesHere switch`
Hier auf das `.#` vor dem `yourHostNameGoesHere` achten. `.#` muss stehen bleiben

## Flakes aktualisieren
``` bash
// Flakes aktualisieren
// muss in '/etc/nixos' ausgeführt werden
nix flake update
```