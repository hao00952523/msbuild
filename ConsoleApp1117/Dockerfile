#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["ConsoleApp1117/ConsoleApp1117.csproj", "ConsoleApp1117/"]
RUN dotnet restore "ConsoleApp1117/ConsoleApp1117.csproj"
COPY . .
WORKDIR "/src/ConsoleApp1117"
RUN dotnet build "ConsoleApp1117.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleApp1117.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "consoleapp1117.dll"]