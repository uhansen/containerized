#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019
ARG source
WORKDIR /inetpub/wwwroot
COPY ${source:-obj/Docker/publish} .


# Install IIS
RUN Install-WindowsFeature Web-Server
RUN Install-WindowsFeature MSMQ-Services
RUN Install-Dtc -LogPath "C:\log" -StartType "AutoStart"

# Expose port 80
# This is important in order for the Azure App Service to pick up the app
EXPOSE 80

# Set the entry point to start IIS
CMD ["C:\\ServiceMonitor.exe", "w3svc"]
