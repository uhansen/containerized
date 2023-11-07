#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019

# Setup Remote IIS management
# RUN powershell Install-WindowsFeature Web-Mgmt-Service; \
# New-ItemProperty -Path HKLM:\software\microsoft\WebManagement\Server -Name EnableRemoteManagement -Value 1 -Force; \
# Set-Service -Name wmsvc -StartupType automatic;

# Install IIS
#RUN Install-WindowsFeature Web-Server

ARG source
WORKDIR /inetpub/wwwroot
COPY ${source:-obj/Docker/publish} .

RUN net user iisadmin P@ssw0rd /add
RUN net localgroup administrators iisadmin /add

# RUN net localgroup "Performance Monitor Users" iisadmin /add
#RUN PowerShell -NoProfile -Command Remove-Item -Recurse C:\inetpub\wwwroot\*

RUN Install-WindowsFeature MSMQ-Services
RUN Install-Dtc -LogPath "C:\log" -StartType "AutoStart"

USER ContainerAdministrator

# Expose port 80
# This is important in order for the Azure App Service to pick up the app
EXPOSE 80
