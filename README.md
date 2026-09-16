# text-repo 
>(All the commands written in this repo can be directly copied and paste in the konsole of the distribution for the it to operate)

This is text based repository to add all necessary texts , commands , and info related to linux  and learnings i do.



# Post Installation Guide For Fedora KDE :-

```Enable parellel downloads and fastest mirror for DNF :-```
>echo -e "max_parellel_downlaods=10\nfastestmirror=True" | sudo tee -a /etc/dnf/dnf.conf


```Fully Update the Base System :-```
>sudo dnf upgrade --refresh -y
>sudo reboot

```Enable Full Flatahub Integration :-```
>flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
>flatapk remote-modify --enable flathub


```Add RPM Fusion Repositories :-```
>sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm 
>sudo dnf install https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm


```Update MetaData :-```
>sudo dnf check-update


```Install NVIDIA propietary drivers & cuda support :-```
>sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
>sudo reboot 
>modinfo -F version nvidia
>nvidia-smi

# vs code integration for fedora kde :-

this contains the commands to configure vscode properly in fedora kde so that it detects my default konsole of fedora and also the username and all the packages related to the coding part like git , python , etc. 

``` Import the repository gpg key :-```

>sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


``` Add the microsoft vs code repository to dnf :-```

>sudo sh -c 'echo -e "[code]\nname=Visual Studio Code \nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https:////packages.micrsosoft.com/keys/micrososft.asc" > /etc/yum.repos.d/vscode.repo'


``` Update system package-cahce :-```

>sudo dnf check-update


``` Install VS Code :-```

>sudo dnf install code


``` Verify the installation :-```

>code --version




# Increase Internet Connectivity :-
this contains necessary steps to increase internet connectivity in fedora kde and stabalize the connection for proper speed and connection been intact throught the work in progress.


1>Disable Wi-Fi Power Saving :-



``` Create a configuration override file :-```

>sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave.conf


``` Paste the following text in the editor :-```


>[connection]

>wifi.powersave = 2


``` Press Ctrl+O to save then enter then  Ctrl+x to exit```


``` Restart Network Manager :-```

>sudo systemctl restart NetworkManager



2>Enable BBR Congestion Control :-

```Linux kernel support  for google's BBR TCP congestion control algorithm improves throughput and network speed over lossy Wi-Fi connections.```


```Open Terminal and Run :-```


>sudo nano /etc/sysctl.d/99-bbr.conf


```Add the following line :-```


>net.core.default_qdisc = fq
>net.ipv4.tcp_congestion_control = bbr


``` Verify BBR is Enabled :-```


>sysctl net.ipv4.tcp_congestion_control



